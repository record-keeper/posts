# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-20T13:30:02.652899+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×41 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×111 (24h)
- 🔴 PSI_DRIFT_DETECTED×41 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-06-20T13:29:00]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×5  [2026-06-20T13:25:38]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 PSI_DRIFT_DETECTED  ×17  [2026-06-20T13:02:35]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-06-20T13:02:35]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-06-20T12:19:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-20T11:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×59  [2026-06-20T10:00:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-20T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S00: n=144 hit%=27.8% hit_CI[Bonf]=[18.4,39.5]% ROI=0.79 ROI_boot95=[0.55,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=136 hit%=29.4% hit_CI[Bonf]=[19.6,41.6]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-20T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=136<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-20T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=35.9% hit_CI[Bonf]=[22.3,52.2]% ROI=0.58 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-20T06:00:16]
- key: `ORPHAN_SCAN|146 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.84 (コスト 10,100/回収 8,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=12.9% ROI=0.21 (コスト 6,900/回収 1,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=31.9% ROI=0.76 (コスト 16,200/回収 12,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=24.3% ROI=1.07 (コスト 8,700/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-20T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=26 hit%=23.1% ROI=0.48 (コスト 7,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.54MB / last modified 2026-06-20T13:30:08.964518+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
ww.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-06-20 13:28:42,212 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=11&hd=20260620: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-06-20 13:28:42,212 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=11&hd=20260620
2026-06-20 13:28:42,212 [ERROR] scraper: racelist fetch failed: jcd=11 rno=7
2026-06-20 13:28:42,212 [WARNING] run_cycle: fetch None: 11/7
2026-06-20 13:28:55,399 [INFO] scraper: odds3t: 120/120 parsed
2026-06-20 13:28:56,519 [INFO] scraper: odds3f: 19/20 parsed
2026-06-20 13:28:57,688 [INFO] scraper: odds2t: 29/30 parsed
2026-06-20 13:28:57,689 [INFO] scraper: odds2f: 11/15 parsed
2026-06-20 13:28:58,772 [INFO] scraper: odds_win: 4/6 parsed
2026-06-20 13:28:58,773 [INFO] scraper: fetch_race 09/7: boats=6 odds=183/191
2026-06-20 13:28:58,784 [INFO] predictor: CALIBRATION_MODE=on
2026-06-20 13:28:58,784 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-06-20 13:28:58,791 [INFO] run_cycle: fetched 09/7 [scan]: 153 combos
2026-06-20 13:28:58,956 [INFO] race_id: notif: nid=2026062009071341 sid=S01_NAKAANA1 phase=scan rank=B
2026-06-20 13:28:59,344 [INFO] notifier: Discord notify OK (status=204)
2026-06-20 13:28:59,918 [INFO] notifier: Discord notify OK (status=204)
2026-06-20 13:29:00,057 [INFO] run_cycle: SCAN S01_NAKAANA1 津7R B
2026-06-20 13:29:00,182 [INFO] run_cycle: run_cycle done: 1 notifications
2026-06-20 13:29:06,986 [INFO] run_cycle: === run_cycle 13:29:06 ===
2026-06-20 13:29:06,986 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-20 13:29:06,986 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-20 13:29:07,058 [INFO] predictor: Models loaded OK
2026-06-20 13:29:07,660 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 102
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 102
  }
]
```

## Phase別通知記録 (24h)
{'final': 44, 'result': 17, 'scan': 41}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 128
  FINAL_MISSING: 111
  PSI_DRIFT_DETECTED: 41
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_SPIKE: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 10 | 9,600 | 8,820 | -780 | 0.919 |
| S01_NAKAANA1 | 30 | 8 | 6,000 | 4,900 | -1,100 | 0.817 |
| S02_TETSUBAN | 14 | 4 | 2,800 | 1,220 | -1,580 | 0.436 |

## 直近アラート (24h・新しい順)
```
[13:29:00] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1189}
[13:27:31] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 6, "baseline_n_days": 7, "baseline_stdev": 2.4, "hour": 13, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 12, "z_score": 2.52}
[13:25:38] FINAL_MISSING: {"deadline": "2026-06-20T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004011155", "sid": "S00"}
[13:25:38] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 6, "baseline_n_days": 7, "baseline_stdev": 2.4, "hour": 13, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 11, "z_score": 2.1}
[13:24:23] FINAL_MISSING: {"deadline": "2026-06-20T12:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062004031254", "sid": "S00"}
[13:06:23] FINAL_MISSING: {"deadline": "2026-06-20T10:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062013011036", "sid": "S00"}
[13:05:31] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 290, "n_recent": 73, "psi": 0.29}
[13:05:31] FINAL_MISSING: {"deadline": "2026-06-20T12:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062005031235", "sid": "S00"}
[13:02:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:01:20] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 290, "n_recent": 72, "psi": 0.292}
```

## 本日残レース: 103件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 65件 締切済
- 通知発射: scan=20 nid / final=21 nid / result=7 nid
- predictions: 12 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 117R | win | 1 | 0.4989 | 12.7 | 6.34 | 300 | scan=- drift=- | 13:27:22 |
| S00 | 065R | win | 1 | 0.5174 | 4.3 | 2.22 | 300 | scan=- drift=- | 13:25:35 |
| S00 | 176R | win | 1 | 0.0754 | 6.0 | 0.45 | 300 | scan=4.5 drift=+33.3% | 13:20:27 |
| S02_TETSUBAN | 136R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 13:05:21 |
| S02_TETSUBAN | 054R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 13:00:54 |
| S00 | 116R | win | 1 | 0.3177 | 13.4 | 4.26 | 300 | scan=16.9 drift=-20.7% | 12:54:32 |
| S02_TETSUBAN | 115R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 12:19:48 |
| S01_NAKAANA1 | 062R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=4.8 drift=-31.2% | 11:55:37 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=4.6 drift=-13.0% | 11:42:21 |
| S00 | 093R | win | 1 | 0.1720 | 11.2 | 1.93 | 300 | scan=12.0 drift=-6.7% | 11:33:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | -5.1% | -61.4% | +43.3% | 17 | 9 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 519.3s |
| **Latency** (scan→final max) | 647.6s |
| **Traffic** (notifications 24h) | 102 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 361 | 0.4717 | 0.2936 | +0.1781 | 🟡+38% | 0.2403 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 144 | 0.4228 | 0.2708 | 0.2216 | 🔴-0.12 | 0.767 |
| S01_NAKAANA1 | win | 139 | 0.4856 | 0.2806 | 0.2443 | 🔴-0.21 | 0.74 |
| S02_TETSUBAN | win | 78 | 0.5372 | 0.3590 | 0.2676 | 🔴-0.16 | 0.585 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 6 | 0.1816 | 0.3333 | 🔴-0.1518 |
| 0.20-0.30 | 10 | 0.2246 | 0.1000 | 🔴+0.1246 |
| 0.30-0.50 | 128 | 0.4199 | 0.2578 | 🔴+0.1621 |
| 0.50+ | 207 | 0.5429 | 0.3333 | 🔴+0.2096 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 44 | 0.711 |
| win | <5.0 | ✅learned | 83 | 0.749 |
| win | <10.0 | ✅learned | 55 | 0.495 |
| win | <20.0 | ✅learned | 15 | 0.207 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-06-20T13:30:02.652899+09:00_