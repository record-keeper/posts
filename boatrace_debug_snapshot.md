# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-21T15:40:01.990766+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×38 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×45 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-21T15:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-11-21T15:23:03]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×4  [2026-11-21T15:23:03]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-11-21T15:23:03]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×10  [2026-11-21T14:48:11]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-21T14:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-21T13:30:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-21T12:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-21T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×19  [2026-11-21T10:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-21T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.0000 gap=+0.1918`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-21T06:00:45]
- key: `ROI_STAT|S00: n=86 hit%=22.1% hit_CI[Bonf]=[12.0,37.1]% ROI=0.60 ROI_boot95=[0.35,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-21T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S00: n=86<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-21T06:00:45]
- key: `ROI_STAT|S01_NAKAANA1: n=105 hit%=26.7% hit_CI[Bonf]=[16.3,40.5]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-21T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=105<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-21T06:00:45]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=40.0% hit_CI[Bonf]=[21.3,62.1]% ROI=0.97 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-21T06:00:45]
- key: `ORPHAN_SCAN|245 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-21T06:00:45]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=25 hit%=20.0% ROI=0.83 (コスト 5,400/回収 4,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-21T06:00:45]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=44 hit%=38.6% ROI=0.84 (コスト 10,200/回収 8,610)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.38MB / last modified 2026-11-21T15:38:46.468110+09:00

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
ry in 1s
2026-11-21 15:38:08,262 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=05&hd=20261121: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-21 15:38:21,570 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=05&hd=20261121: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-21 15:38:21,570 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=05&hd=20261121
2026-11-21 15:38:31,780 [INFO] scraper: odds2t: 30/30 parsed
2026-11-21 15:38:31,781 [INFO] scraper: odds2f: 15/15 parsed
2026-11-21 15:38:41,886 [INFO] scraper: odds_win: 6/6 parsed
2026-11-21 15:38:41,887 [INFO] scraper: fetch_race 05/12: boats=6 odds=171/191
2026-11-21 15:38:41,889 [INFO] predictor: CALIBRATION_MODE=on
2026-11-21 15:38:41,889 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-21 15:38:41,894 [INFO] run_cycle: fetched 05/12 [scan]: 156 combos
2026-11-21 15:38:42,093 [INFO] run_cycle: run_cycle done: 1 notifications
2026-11-21 15:39:05,030 [INFO] run_cycle: === run_cycle 15:39:05 ===
2026-11-21 15:39:05,030 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-21 15:39:05,030 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-21 15:39:05,133 [INFO] predictor: Models loaded OK
2026-11-21 15:39:33,672 [INFO] scraper: odds3t: 120/120 parsed
2026-11-21 15:39:43,819 [INFO] scraper: odds3f: 20/20 parsed
2026-11-21 15:39:54,869 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=24&hd=20261121: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-21 15:40:04,681 [INFO] scraper: odds2t: 28/30 parsed
2026-11-21 15:40:04,684 [INFO] scraper: odds2f: 15/15 parsed

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
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 7, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  FINAL_MISSING: 45
  PSI_DRIFT_DETECTED: 38
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 9 | 3 | 2,700 | 1,860 | -840 | 0.689 |
| S01_NAKAANA1 | 17 | 6 | 3,400 | 2,920 | -480 | 0.859 |
| S02_TETSUBAN | 6 | 4 | 1,200 | 2,720 | +1,520 | 2.267 |

## 直近アラート (24h・新しい順)
```
[15:38:42] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 190, "n_recent": 32, "psi": 0.474}
[15:38:42] FINAL_MISSING: {"deadline": "2026-11-21T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112102061300", "sid": "S00"}
[15:38:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 481}
[15:33:11] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 475}
[15:28:23] FINAL_MISSING: {"deadline": "2026-11-21T11:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112122031149", "sid": "S00"}
[15:28:23] FINAL_MISSING: {"deadline": "2026-11-21T12:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112105061252", "sid": "S01_NAKAANA1"}
[15:28:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[15:22:59] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:13:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[15:08:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 489}
```

## 本日残レース: 51件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 117件 締切済
- 通知発射: scan=20 nid / final=13 nid / result=7 nid
- predictions: 7 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 136R | win | 1 | 0.5891 | 4.8 | 2.83 | 300 | scan=- drift=- | 12:57:00 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=- drift=- | 12:44:23 |
| S01_NAKAANA1 | 045R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=- drift=- | 12:38:22 |
| S02_TETSUBAN | 135R | win | 1 | 0.5174 | 2.7 | 1.40 | 200 | scan=2.7 drift=+0.0% | 12:29:13 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.1 drift=+4.9% | 11:37:25 |
| S00 | 042R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=- drift=- | 11:17:13 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5891 | 3.1 | 1.83 | 200 | scan=- drift=- | 10:59:24 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.8 drift=-25.0% | 12:53:02 |
| S01_NAKAANA1 | 218R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 12:08:26 |
| S01_NAKAANA1 | 0410R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.1 drift=+6.5% | 15:03:39 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 15 | +0.3% | -26.8% | +55.6% | 6 | 0 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 324.7s |
| **Latency** (scan→final max) | 510.8s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 222 | 0.4761 | 0.3063 | +0.1698 | 🟡+36% | 0.2330 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 84 | 0.4335 | 0.2500 | 0.2125 | 🔴-0.13 | 0.671 |
| S01_NAKAANA1 | win | 98 | 0.4827 | 0.3061 | 0.2370 | 🔴-0.12 | 0.784 |
| S02_TETSUBAN | win | 40 | 0.5496 | 0.4250 | 0.2661 | 🔴-0.09 | 1.183 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 90 | 0.4107 | 0.2778 | 🔴+0.1330 |
| 0.50+ | 123 | 0.5461 | 0.3496 | 🔴+0.1966 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 208 | 0.818 |
| win | <5.0 | ✅learned | 378 | 0.737 |
| win | <10.0 | ✅learned | 160 | 0.449 |
| win | <20.0 | ✅learned | 48 | 0.252 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-11-21T15:40:01.990766+09:00_