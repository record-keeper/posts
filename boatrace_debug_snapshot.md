# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-26T11:30:02.442345+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×109 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-05-26T11:20:26]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 KS_ODDS_DRIFT  ×13  [2026-05-26T11:17:38]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-05-26T11:09:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-05-26T11:01:49]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-05-26T10:37:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-05-26T10:00:09]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-05-26T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-26T06:00:11]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.3333 gap=-0.1090`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=32.7% ROI=0.88 (コスト 14,500/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S00: n=183 hit%=27.3% hit_CI[Bonf]=[19.0,37.7]% ROI=0.91 ROI_boot95=[0.66,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=81 hit%=27.2% hit_CI[Bonf]=[15.5,43.0]% ROI=0.71 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=45 hit%=46.7% hit_CI[Bonf]=[27.5,66.9]% ROI=0.86 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=45<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=25.6% ROI=0.94 (コスト 9,000/回収 8,440)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=65 hit%=27.7% ROI=0.85 (コスト 15,700/回収 13,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=27 hit%=25.9% ROI=1.03 (コスト 6,600/回収 6,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.54MB / last modified 2026-05-26T11:30:05.300736+09:00

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
11:28:31,884 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-05-26 11:28:31,891 [INFO] run_cycle: fetched 13/3 [final]: 154 combos
2026-05-26 11:28:34,467 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=2
2026-05-26 11:28:34,467 [WARNING] run_cycle: fetch None: 03/2
2026-05-26 11:28:34,467 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-26 11:29:05,667 [INFO] run_cycle: === run_cycle 11:29:05 ===
2026-05-26 11:29:05,667 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 11:29:05,667 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 11:29:05,733 [INFO] predictor: Models loaded OK
2026-05-26 11:29:16,801 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260526: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-26 11:29:27,864 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260526: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-05-26 11:29:42,278 [INFO] scraper: odds3t: 120/120 parsed
2026-05-26 11:29:43,404 [INFO] scraper: odds3f: 20/20 parsed
2026-05-26 11:29:44,595 [INFO] scraper: odds2t: 29/30 parsed
2026-05-26 11:29:44,596 [INFO] scraper: odds2f: 14/15 parsed
2026-05-26 11:29:45,675 [INFO] scraper: odds_win: 6/6 parsed
2026-05-26 11:29:45,676 [INFO] scraper: fetch_race 13/3: boats=6 odds=189/191
2026-05-26 11:29:45,680 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 11:29:45,680 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-05-26 11:29:45,684 [INFO] run_cycle: fetched 13/3 [final]: 155 combos
2026-05-26 11:29:48,344 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=2
2026-05-26 11:29:48,344 [WARNING] run_cycle: fetch None: 03/2
2026-05-26 11:29:48,344 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 34
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 34
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 8, 'scan': 14}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 109
  FINAL_MISSING: 109
  ANOMALY_SCAN_FINAL_RATIO: 26
  KS_ODDS_DRIFT: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 11 | 10,500 | 13,320 | +2,820 | 1.269 |
| S01_NAKAANA1 | 33 | 7 | 6,600 | 5,080 | -1,520 | 0.77 |
| S02_TETSUBAN | 13 | 6 | 2,600 | 1,980 | -620 | 0.762 |

## 直近アラート (24h・新しい順)
```
[11:20:26] SEND_WITHOUT_DBREC: {"kind": "SEND_WITHOUT_DBREC", "nid": "2026052610061050", "phase": "result", "sid": "S00"}
[11:17:38] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.009125, "ks_stat": 0.209}
[11:17:38] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.347, "baseline_mean": 0.847, "baseline_stdev": 0.144, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -2.41}
[11:12:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.597, "baseline_mean": 0.847, "baseline_stdev": 0.144, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 4, "z_score": -4.15}
[11:09:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.514, "baseline_mean": 0.847, "baseline_stdev": 0.144, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -3.57}
[11:01:48] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:37:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 673}
[10:36:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 652}
[10:35:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 655}
[10:34:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 647}
```

## 本日残レース: 104件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 28件 締切済
- 通知発射: scan=4 nid / final=4 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 106R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:47:22 |
| S01_NAKAANA1 | 1210R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 19:39:21 |
| S00 | 126R | win | 1 | 0.5123 | 5.6 | 2.87 | 300 | scan=- drift=- | 17:56:33 |
| S01_NAKAANA1 | 039R | win | 1 | 0.5891 | 3.1 | 1.83 | 200 | scan=3.0 drift=+3.3% | 14:50:24 |
| S02_TETSUBAN | 056R | win | 1 | 0.5226 | 2.0 | 1.05 | 200 | scan=- drift=- | 14:09:21 |
| S00 | 034R | win | 1 | 0.0295 | 5.9 | 0.17 | 300 | scan=14.2 drift=-58.5% | 12:32:22 |
| S01_NAKAANA1 | 132R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.1 drift=+17.1% | 11:07:21 |
| S00 | 132R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.1 drift=+17.1% | 11:07:21 |
| S01_NAKAANA1 | 236R | win | 1 | 0.5174 | 3.7 | 1.91 | 200 | scan=- drift=- | 10:43:20 |
| S00 | 102R | win | 1 | 0.0918 | 5.6 | 0.51 | 300 | scan=5.4 drift=+3.7% | 09:02:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +2.1% | -78.6% | +157.5% | 18 | 10 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 508.5s |
| **Latency** (scan→final max) | 644.5s |
| **Traffic** (notifications 24h) | 34 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 308 | 0.4551 | 0.2987 | +0.1564 | 🟡+34% | 0.2310 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4279 | 0.2692 | 0.2195 | 🔴-0.12 | 0.899 |
| S01_NAKAANA1 | win | 81 | 0.4857 | 0.2716 | 0.2446 | 🔴-0.24 | 0.71 |
| S02_TETSUBAN | win | 45 | 0.5101 | 0.4667 | 0.2534 | 🔴-0.02 | 0.858 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 136 | 0.4185 | 0.2426 | 🔴+0.1758 |
| 0.50+ | 146 | 0.5402 | 0.3699 | 🔴+0.1703 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 21 | 0.761 |
| win | <5.0 | ✅learned | 38 | 0.802 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-26T11:30:02.442345+09:00_