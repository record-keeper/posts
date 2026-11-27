# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-27T15:50:02.036227+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×27 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×107 (24h)
- 🔴 PSI_DRIFT_DETECTED×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-11-27T15:25:13]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-11-27T15:06:21]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T15:00:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-11-27T14:51:15]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-27T14:30:08]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-11-27T13:19:37]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T13:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-27T12:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-11-27T09:01:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S00: n=55 hit%=16.4% hit_CI[Bonf]=[6.7,34.9]% ROI=0.44 ROI_boot95=[0.17,0.78]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=55<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=80 hit%=33.8% hit_CI[Bonf]=[20.7,49.9]% ROI=0.90 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=38 hit%=42.1% hit_CI[Bonf]=[22.5,64.5]% ROI=0.93 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=38<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-27T06:00:12]
- key: `ORPHAN_SCAN|282 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-27T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=34 hit%=50.0% ROI=1.33 (コスト 7,700/回収 10,210)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|bt=win: n=173 pred=0.4718 actual=0.3006 error=+0.1712 (+36%) brier=0.2335 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.79MB / last modified 2026-11-27T15:45:28.801659+09:00

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
craper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=2&jcd=15&hd=20261127: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-27 15:48:22,469 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds3f?rno=2&jcd=15&hd=20261127
2026-11-27 15:48:33,502 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=2&jcd=15&hd=20261127: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-27 15:48:42,657 [INFO] scraper: odds2t: 29/30 parsed
2026-11-27 15:48:42,658 [INFO] scraper: odds2f: 15/15 parsed
2026-11-27 15:48:53,670 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=2&jcd=15&hd=20261127: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-27 15:49:02,846 [INFO] scraper: odds_win: 2/6 parsed
2026-11-27 15:49:02,846 [INFO] scraper: fetch_race 15/2: boats=6 odds=166/191
2026-11-27 15:49:02,850 [INFO] predictor: CALIBRATION_MODE=on
2026-11-27 15:49:02,850 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-11-27 15:49:02,853 [INFO] run_cycle: fetched 15/2 [scan]: 151 combos
2026-11-27 15:49:14,014 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=02&hd=20261127: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-27 15:49:25,075 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=02&hd=20261127: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-27 15:49:47,329 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=12&jcd=02&hd=20261127: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

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
    "c": 43
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 43
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 9, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 214
  FINAL_MISSING: 107
  PSI_DRIFT_DETECTED: 27
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 15 | 3 | 4,500 | 2,190 | -2,310 | 0.487 |
| S01_NAKAANA1 | 24 | 11 | 4,800 | 5,600 | +800 | 1.167 |
| S02_TETSUBAN | 11 | 6 | 2,200 | 3,560 | +1,360 | 1.618 |

## 直近アラート (24h・新しい順)
```
[15:43:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 487}
[15:43:47] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.228, "baseline_mean": 0.5, "baseline_stdev": 0.093, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.273, "today_scan_count": 11, "z_score": -2.44}
[15:35:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 471}
[15:29:43] FINAL_MISSING: {"deadline": "2026-11-27T12:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112713061257", "sid": "S02_TETSUBAN"}
[15:29:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 462}
[15:25:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:25:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 478}
[15:17:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 484}
[15:12:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 483}
[15:06:13] FINAL_MISSING: {"deadline": "2026-11-27T12:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112702051233", "sid": "S00"}
```

## 本日残レース: 55件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 101件 締切済
- 通知発射: scan=11 nid / final=6 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 072R | win | 1 | 0.5735 | 3.6 | 2.06 | 200 | scan=4.3 drift=-16.3% | 15:45:24 |
| S02_TETSUBAN | 039R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:28:27 |
| S01_NAKAANA1 | 033R | win | 1 | 0.5703 | 4.8 | 2.74 | 200 | scan=- drift=- | 11:50:46 |
| S00 | 033R | win | 1 | 0.5703 | 4.8 | 2.74 | 300 | scan=- drift=- | 11:50:34 |
| S02_TETSUBAN | 131R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=2.6 drift=-3.8% | 10:35:36 |
| S00 | 235R | win | 1 | 0.5312 | 4.7 | 2.50 | 300 | scan=6.1 drift=-23.0% | 10:31:14 |
| S01_NAKAANA1 | 206R | win | 1 | 0.5047 | 3.0 | 1.51 | 200 | scan=- drift=- | 17:28:06 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.0 drift=+20.0% | 16:53:40 |
| S02_TETSUBAN | 0312R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.4 drift=+0.0% | 15:59:32 |
| S01_NAKAANA1 | 192R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:45:15 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 22 | +10.6% | -58.9% | +114.7% | 6 | 2 | 17 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 362.2s |
| **Latency** (scan→final max) | 551.0s |
| **Traffic** (notifications 24h) | 43 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 169 | 0.4726 | 0.3077 | +0.1649 | 🟡+35% | 0.2333 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 55 | 0.4104 | 0.1636 | 0.1923 | 🔴-0.41 | 0.458 |
| S01_NAKAANA1 | win | 77 | 0.4829 | 0.3506 | 0.2442 | 🔴-0.07 | 0.934 |
| S02_TETSUBAN | win | 37 | 0.5435 | 0.4324 | 0.2717 | 🔴-0.11 | 0.943 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 67 | 0.4093 | 0.2985 | 🔴+0.1108 |
| 0.50+ | 95 | 0.5431 | 0.3368 | 🔴+0.2062 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 213 | 0.817 |
| win | <5.0 | ✅learned | 387 | 0.739 |
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
_auto-generated by claude_snapshot.py at 2026-11-27T15:50:02.036227+09:00_